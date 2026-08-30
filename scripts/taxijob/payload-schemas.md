# Payload Schemas

Shared type contracts used across callbacks and events.

```ts
type Mission = {
  id: string;
  code: string;
  stationId: string;
  status: 'waiting' | 'offered' | 'assigned' | 'pickup' | 'awaiting-meter' | 'in-progress' | 'completed' | 'failed';
  titleId: string;
  type: 'taxi-call';
  priority: 'high';
  pickup: Point;
  destination: Point;
  pickupArea: string;
  passengerCount: 1;
  estimatedDistanceKm: number;
  estimatedFare: number;
  estimatedMinutes: number;
  waitSeconds: number;
  distanceKm: number;
  fare: number;
  tip: number;
  npcNetId?: number;
  vehicleNetId?: number;
  driverIdentifier?: string;
  driverName?: string;
  assignedEmployeeId?: string;
  waypoint: boolean;
  createdAt: number;
  offeredAt?: number;
  acceptedAt?: number;
  meterStartedAt?: number;
  statusChangedAt: number;
  expiresAt?: number;
};

type Point = { index: number; label: string; address: string; coords: { x: number; y: number; z: number } };

type Meter = {
  missionId: string;
  manual?: true;
  visibility: 'open' | 'closed';
  state: 'idle' | 'active' | 'completed' | 'error';
  canControl: boolean;
  actualFare: number;
  actualDistance: number;
  distanceUnit: 'km' | 'mile';
  vehicleNetId: number;
  updatedAt: number;
  passengers?: Array<{ source: number; name: string; inVehicle: true }>;
};

type Invoice = {
  id: string;
  amount: number;
  expiresAt: number;
  bankBalance: number | null;
  cashBalance: number | null;
};

type EmploymentInvitation = {
  id: string;
  managerSource: number;
  managerName: string;
  stationName: string;
  expiresAt: number;
  durationSeconds: number;
};
```

### Vehicle states

Fleet vehicles are always in one of three states:

| State       | Meaning                                     |
| ----------- | ------------------------------------------- |
| `garage`    | Stored, ready to deploy                     |
| `in-use`    | Currently deployed by an employee           |
| `impounded` | Impounded — recoverable via `payImpoundFee` |

`DeployPayload` (sent with `vehicleSpawned`) contains at least `vehicleId`, `networkId`, `plate`, `model` and the vehicle `properties`.

### UI Snapshot

The `snapshot` returned by `bootstrap` and delivered by `stateChanged` shares one contract:

```ts
type Snapshot = {
  station: {
    id: string;
    label: string;
    job: string;
    purchased: boolean;
    ownerIdentifier: string | null;
    purchasedAt: number | null;
  };
  currentPlayerIdentifier: string | null;
  permissions: { employee: boolean; manager: boolean };
  employees: unknown[];
  vehicles: unknown[];
  ownedVehicles: unknown[];       // management view only
  purchasableVehicles: unknown[]; // management view only
  missions: Mission[];
  progression: {
    currentLevel: number;
    currentXp: number;
    nextLevelXp: number;
    employeeCapacity: number;
    vehicleCapacity: number;
    milestones: Array<{ level: number; requiredTrips: number; employeeCapacity: number; vehicleCapacity: number }>;
  };
  contract: {
    stationId: string; stationName: string; location: string; purchasePrice: number;
    startingCapacity: number; includedVehicles: { count: number; model: string };
    buyerName: string; signed: false; signedAtIso: null;
  };
  meter: Meter | null;
  vault: { balance: number; todayIncome: number; todayExpenses: number; transactions: unknown[] };
  automaticAssignment: boolean;
  revision: number;
  serverTime: string;
};
```

**View scoping:** in `employee-menu` views, `employees` contains only the caller and `missions` only the caller's missions. In non-management views, `ownedVehicles` and `purchasableVehicles` are empty and `vault` is zeroed.
